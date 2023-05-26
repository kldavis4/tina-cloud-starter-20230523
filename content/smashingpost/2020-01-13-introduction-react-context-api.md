---
title: 'An Introduction To React’s Context API'
slug: introduction-react-context-api
author: yusuff-faruq
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db3ed2a5-7a94-4bab-a9f5-275d1ca394f0/introduction-react-context-api.png
date: 2020-01-13T11:30:00.000Z
summary: >-
  In this article, you will learn how to use React’s Context API which allows you to manage global application states in your React apps without resorting to props drilling.
description: >-
  In this article, you will learn how to use React’s Context API which allows you to manage global application states in your React apps without resorting to props drilling.
categories:
  - API
  - React
  - Apps
---

For this tutorial, you should have a fair understanding of hooks. Still, before we begin, I’ll briefly discuss what they are and the hooks we’ll be using in this article.

According to the [React Docs](https://reactjs.org/docs/hooks-state.html):

<blockquote>“<em>Hooks</em> are a new addition in React 16.8. They let you use state and other React features without writing a class.”</blockquote>

That is basically what a React hook is. It allows us to use state, refs and other React features in our functional components.

Let us discuss the two hooks we will encounter in this article.

### The `useState` Hook

The useState hook **allows us to use state** in our functional components. A `useState` hook takes the initial value of our state as the only argument, and it returns an array of two elements. The first element is our state variable and the second element is a function in which we can use the update the value of the state variable.

Let’s take a look at the following example:

<pre><code class="language-javascript">import React, {useState} from "react";

function SampleComponent(){
   const [count, setCount] = useState(0);
}
</code></pre>

Here, `count` is our state variable and its initial value is `0` while `setCount` is a function which we can use to update the value of count.

### The `useContext` Hook

I will discuss this later in the article but this hook basically **allows us to consume** the value of a context. What this actually means will become more apparent later in the article.

<div class="c-felix-the-cat">
<h4 class="h3">Yarn Workspaces</h4>
<p>Yarn workspaces let you organize your project codebase using a monolithic repository (monorepo). React is a good example of an open-source project that is monorepo and uses Yarn workspaces to achieve that purpose. <a href="https://www.smashingmagazine.com/2019/07/yarn-workspaces-organize-project-codebase-pro/" class="btn btn--medium btn--blue">Read a related article&nbsp;&rarr;</a></p>
</div>

{{% feature-panel %}}

## Why Do We Need The Context API?

We want to build a “theme toggler” component which toggles between light mode and dark mode for our React app. Every component has to have access to the current theme mode so they can be styled accordingly.

Normally, we would provide the current theme mode to all the components through props and update the current theme using `state`:

<pre><code class="language-javascript">import React from "react";
import ReactDOM from "react-dom";

function App() {
  return (
    &lt;div&gt;
      &lt;Text theme= "blue" /&gt;
      &lt;h1&gt;{theme}&lt;/h1&gt;
    &lt;/div&gt;
  );
}

function Text({theme}) {
return(
  &lt;h1 style = {{
     color: `${theme}`
  }}&gt;{theme}&lt;/h1&gt;
);
}

const rootElement = document.getElementById("root");
ReactDOM.render(&lt;App /&gt;, rootElement);
</code></pre>

In the code sample above, we created a Text Component which renders an `h1` element. The color of the `h1` element depends on the current theme mode. Currently, the theme is blue. We can toggle between `blue` and `red` themes by using `state`.

We will create a state called “theme” using the `useState` hook. The `useState` hook will return the current value of the theme and a function which we can use to update the theme.

So, let us create our theme state:

<pre><code class="language-javascript">const [theme, setTheme] = React.useState("blue");
</code></pre>

We will also add a button element to our `App` component. This button will be used to toggle the themes and it needs a click event handler. So, let us write the click event handler like so:

<pre><code class="language-javascript">const onClickHandler = () => {
  setTheme();
}
</code></pre>

Now, we want to set the new theme to `Red` if the current theme is `Blue`, and vice versa. Instead of using an `if` statement, a more convenient way to do this is with the help of the ternary operator in JavaScript.

<pre><code class="language-javascript">setTheme( theme === "red"? "blue": "red");
</code></pre>

So now, we have written our `onClick` handler. Let’s add this button element to the `App` component:

<pre><code class="language-javascript">&lt;button onClick = {onClickHandler}&gt;Change theme&lt;/button&gt;
</code></pre>

Let us also change the value of the theme props of the Text component to the theme state.

<pre><code class="language-javascript">&lt;Text theme={theme}/&gt;
</code></pre>

Now, we should have this:

<pre><code class="language-javascript">import React from "react";
import ReactDOM from "react-dom";

import "./styles.css";


function App() {
  const[theme, setTheme] = React.useState("red");

  const onClickHandler = () =&gt; {
  setTheme( theme === "red"? "blue": "red");
  }

  return (
    &lt;div&gt;
      &lt;Text theme={theme}/&gt;
      &lt;button onClick = {onClickHandler}&gt;Change theme&lt;/button&gt;
    &lt;/div&gt;
  );
}

function Text({theme}) {
return(
  &lt;h1 style = {{
     color: `${theme}`
  }}&gt;{theme}&lt;/h1&gt;
);
}

const rootElement = document.getElementById("root");
ReactDOM.render(&lt;App /&gt;, rootElement);
</code></pre>

We can now toggle between our two themes. However, if this was a much larger application, it would be difficult to use the theme in deeply nested components and the code becomes unwieldy.

## Introducing The Context API

Let me introduce the Context API. According to the React documentation:

<blockquote>“Context provides a way to pass data through the component tree without having to pass props down manually at every level.”</blockquote>

For a more in-depth definition, it provides a way for you to make particular data available to all components throughout the component tree no matter how deeply nested that component may be.

Let us look at this example:

<pre><code class="language-javascript">const App = () =&gt; {
  return(
    &lt;ParentComponent theme = "light"/&gt;
  );
}

const ParentComponent = (props) =&gt; (
  &lt;Child theme = {props.theme} /&gt;
)

const Child = (props) =&gt; (
  &lt;Grandchild theme = {props.theme} /&gt;
)

const Grandchild = (props) =&gt; (
  &lt;p&gt;Theme: {props.theme}&lt;/p&gt;
)
</code></pre>

In the example above, we specified the application theme using a props in the `ParentComponent` called `theme`. We had to pass that props to all components down the component tree to get it where it is needed which is the `GrandChild` component. The `ChildComponent` had nothing to do with the theme props but was just used as an intermediary.

Now, imagine the `GrandChild` component was more deeply nested than it was in the top example. We would have to pass the theme props the same way we did here which would be cumbersome. This is the problem that `Context` solves. With `Context`, every component in the component tree has access to whatever data we decide to put in our context.

{{% ad-panel-leaderboard %}}

## Let’s Get Started With `Context`

It’s time to replicate the theme toggling button we built at the beginning of the article with the Context API. This time, our theme toggler will be a separate component. We will build a `ThemeToggler` component which switches the theme of our React app using `Context`.

First, let us initialize our React app. (I prefer using `create-react-app` but you can use whatever method you prefer.)

Once you have initialized your React project, create a file called *ThemeContext.js* in your `/src` folder. You can also create a folder called `/context` and place your *ThemeContext* file in there if you want.

Now, let us move on.

### Creating Your Context API

We will create our theme context in our *ThemeContext.js* file.

To create a context, we use `React.createContext` which creates a context object. You can pass in anything as an argument to `React.createContext`. In this case, we are going to pass in a string which is the current theme mode. So now our current theme mode is the “light” theme mode.

<pre><code class="language-javascript">import React from "react";

const ThemeContext = React.createContext("light");
export default ThemeContext;
</code></pre>

To make this context available to all our React components, we have to use a Provider. What is a Provider? According to the React documentation, **every context object comes with a Provider React component** that allows consuming components to subscribe to context changes. It is the provider that allows the context to be consumed by other components. That said, let us create our provider.

Go to your *App.js* file. In order to create our provider, we have to import our `ThemeContext`.

Once the `ThemeContext` has been imported, we have to enclose the contents of our `App` component in `ThemeContext.Provider` tags and give the `ThemeContext.Provider` component a props called `value` which will contain the data we want to make available to our component tree.

<pre><code class="language-javascript">function App() {
  const theme = "light";
  return (
    &lt;ThemeContext.Provider value = {theme}&gt;
      &lt;div&gt;
      &lt;/div&gt;
    &lt;/ThemeContext.Provider&gt;
  );
}
</code></pre>

So now the value of “light” is available to all our components (which we will write soon).

{{% ad-panel-leaderboard %}}

## Creating Our Theme File

Now, we will create our theme file that will contain the different color values for both our light and dark themes. Create a file in your `/src` folder called *Colors.js*.

In *Colors.js*, we will create an object called `AppTheme`. This object will contain the colors for our themes. Once you are done, export the `AppTheme` object like so:

<pre><code class="language-javascript">const AppTheme = {
    light: {
        textColor: "#000",
        backgroundColor: "#fff"
    },
    dark: {
        textColor: "#fff",
        backgroundColor: "#333"
    }
}

export default AppTheme;
</code></pre>

Now it’s time to start creating our different React components.

{{% ad-panel-leaderboard %}}

## Creating Our React Components

Let’s create the following components:

- `Header`
- `ThemeToggler`
- `MainWithClass`

#### Header.jsx

<pre><code class="language-javascript">import React from "react";
import ThemeToggler from "./ThemeToggler";

const headerStyles = {
    padding: "1rem",
    display: "flex",
    justifyContent: "space-between",
    alignItems: "center"
}
const Header = () =&gt; {
    return(
        &lt;header style = {headerStyles}&gt;
            &lt;h1&gt;Context API&lt;/h1&gt;
            &lt;ThemeToggler /&gt;
        &lt;/header&gt;
    );
}

export default Header;
</code></pre>

#### ThemeToggler.jsx

(For now, we will just return an empty `div`.)

<pre><code class="language-javascript">import React from "react";
import ThemeContext from "../Context/ThemeContext";

const themeTogglerStyle = {
    cursor: "pointer"
}
const ThemeToggler = () =&gt; {
        return(
            &lt;div style = {themeTogglerStyle}&gt;
            &lt;/div&gt;
    );
}

export default ThemeToggler;
</code></pre>

### Consuming Context With Class-Based Components

Here, we will use the value of our `ThemeContext`. As you may already know, we have **two methods of writing components in React**: through functions or classes. The process of use context in both methods is different so we will create two components to serve as the main section of our application: `MainWithClass` and `MainWithFunction`.

Let us start with `MainWithClass`.

#### MainWithClass.jsx

We will have to import our `ThemeContext` and `AppTheme`. Once that is done, we will write a class that returns our JSX from a render method. Now we have to consume our context. There are two methods to do this with class-based components:

<ol><li>The first method is through <code>Class.contextType</code>.<br /><br />To use this method, we assign the context object from our <code>ThemeContext</code> to <code>contextType</code> property of our class. After that, we will be able to access the context value using <code>this.context</code>. You can also reference this in any of the lifecycle methods and even the render method.<br /><br /> 

<pre><code class="language-javascript">import React, { Component } from "react";
import ThemeContext from "../Context/ThemeContext";
import AppTheme from "../Colors";

class Main extends Component{
    constructor(){
        super();
    }
    static contextType = ThemeContext;
    render(){
        const currentTheme = AppTheme[this.context];
        return(
            &lt;main&gt;&lt;/main&gt;
        );
    }

}
</code></pre>

<br />After assigning <code>ThemeContext</code> to the <code>contextType</code> property of our class, I saved the current theme object in the <code>currentTheme</code> variable.<br /><br />Now, we will grab the colors from the <code>currentTheme</code> variable and use them to style some markup.<br />

<pre><code class="language-javascript">render() {
        const currentTheme = AppTheme[this.context];
        return (
            &lt;main style={{
                padding: "1rem",
                backgroundColor: `${currentTheme.backgroundColor}`,
                color: `${currentTheme.textColor}`,

            }}&gt;
                &lt;h1&gt;Heading 1&lt;/h1&gt;
                &lt;p&gt;This is a paragraph&lt;/p&gt;
                &lt;button&gt; This is a button&lt;/button&gt;
            &lt;/main&gt;
</code></pre>

<br />That’s it! This method, however, limits you to consuming only one context.</li>

<li>The second method is <code>ThemeContext.Consumer</code> that involves the use of a Consumer. Each context object also comes with a Consumer React component which can be used in a class-based component. The consumer component takes a child as a function and that function returns a React node. The current context value is passed to that function as an argument.<br /><br />Now, let us replace the code in our <code>MainWithClass</code> component with this:<br />

<div class="break-out">

 <pre><code class="language-javascript">class Main extends Component {
    constructor() {
        super();
        this.state = {
        }
    }
    render(){
               return(
                    &lt;ThemeContext.Consumer&gt;
                   {
                    (theme) =&gt; {
                        const currentTheme = AppTheme[theme];
                        return(
                            &lt;main style = {{
                                padding: "1rem",
                                backgroundColor: `${currentTheme.backgroundColor}`,
                                color: `${currentTheme.textColor}`,
                            
                            }}&gt;
                                &lt;h1&gt;Heading 1&lt;/h1&gt;
                                &lt;p&gt;This is a paragraph&lt;/p&gt;
                                &lt;button&gt; This is a button&lt;/button&gt;
                            &lt;/main&gt;
                        )
                       
                    }
                }
            &lt;/ThemeContext.Consumer&gt;
        );
    }

}
</code></pre>
</div>

<br />As you can see, we used the current value of our <code>ThemeContext</code> which we aliased as “theme” and we grabbed the color values for that theme mode and assigned it to the variable <code>currentTheme</code>. With this method, you can use multiple Consumers.</li>
</ol>

Those are the two methods of consuming context with class-based components.

### Consuming Context With Functional Components

Consuming context with functional components is easier and less tedious than doing so with class-based components. To consume context in a functional component, we will use a hook called `useContext`.

Here is what consuming our `ThemeContext` with a functional component would look like:

<pre><code class="language-javascript">const Main = () =&gt; {
    const theme = useContext(ThemeContext);
    const currentTheme = AppTheme[theme];
    return(
        &lt;main style = {{
            padding: "1rem",
            backgroundColor: `${currentTheme.backgroundColor}`,
            color: `${currentTheme.textColor}`,
        
        }}&gt;
            &lt;h1&gt;Heading 1&lt;/h1&gt;
            &lt;p&gt;This is a paragraph&lt;/p&gt;
            &lt;button&gt; This is a button&lt;/button&gt;
        &lt;/main&gt;
    );
}

export default Main;
</code></pre>

As you can see, all we had to do was use our `useContext` hook with our `ThemeContext` passed in as an argument.

**Note**: *You have to use these different components in the App.js file in order to see the results.*

## Updating Our Theme With The `ThemeToggler` Component

Now we are going to work on our `ThemeToggler` component. We need to be able to switch between the light and dark themes. To do this, we are going to need to edit our *ThemeContext.js*. Our `React.createContext` will now take an object resembling the result of a `useState` hook as an argument.

<pre><code class="language-javascript">const ThemeContext = React.createContext(["light", () =&gt; {}]);
</code></pre>

We passed an array to the `React.createContext` function. The first element in the array is the current theme mode and the second element is the function that would be used to update the theme. As I said, this just resembles the result of a `useState` hook but it is not exactly the result of a `useState` hook.

Now we will edit our *App.js* file. We need to change the value passed to the provider to a `useState` hook. Now the value of our Theme Context is a `useState` hook whose default value is “light”.

<pre><code class="language-javascript">function App() {
  const themeHook = useState("light");
  return (
    &lt;ThemeContext.Provider value = {themeHook}&gt;
      &lt;div&gt;
        &lt;Header /&gt;
        &lt;Main /&gt;
        
      &lt;/div&gt;
    &lt;/ThemeContext.Provider&gt;
  );
}
</code></pre>

### Writing Our `ThemeToggler` Component

Let us now actually write our `ThemeToggler` component:

<div class="break-out">

 <pre><code class="language-javascript">import React,{useContext} from "react";
import ThemeContext from "../Context/ThemeContext";

const themeTogglerStyle = {
    cursor: "pointer"
}
const ThemeToggler = () =&gt; {
    const[themeMode, setThemeMode] = useContext(ThemeContext);
    return(
        &lt;div style = {themeTogglerStyle} onClick = {() =&gt; {setThemeMode(themeMode === "light"? "dark": "light")}}&gt;
            &lt;span title = "switch theme"&gt;
                {themeMode === "light" ? "🌙" : "☀️"}
            &lt;/span&gt;
        &lt;/div&gt;
    );
}

export default ThemeToggler;
</code></pre>
</div>

Since the value of our theme context is now a hook whenever we call `useContext` on it, it will return an array. Using destructuring, we were able to grab the elements from the array. We then wrote an `onClick` event handler for our `ThemeToggler`. With that code, whenever the theme toggler is clicked, it will switch the theme of our application.

Now we will edit the different versions of our `Main` component.

### Editing Our `MainWithClass` Component

<ol>
  <li>The version of the <code>MainWithClass</code> component that uses the <code>Class.contextType</code> method:<br />

<div class="break-out">

 <pre><code class="language-javascript">import React, { Component } from "react";
import ThemeContext from "../Context/ThemeContext";
import AppTheme from "../Colors";

class Main extends Component{
    constructor(){
        super();
    }
    static contextType = ThemeContext;
    render(){
        const currentTheme = AppTheme[this.context[0]];
        return(
            &lt;main style={{
                padding: "1rem",
                backgroundColor: `${currentTheme.backgroundColor}`,
                color: `${currentTheme.textColor}`,

            }}&gt;
                &lt;h1&gt;Heading 1&lt;/h1&gt;
                &lt;p&gt;This is a paragraph&lt;/p&gt;
                &lt;button&gt; This is a button&lt;/button&gt;
            &lt;/main&gt;

        );
    }

}
</code></pre>
</div>
</li>
<li>The version of the <code>MainWithClass</code> component that uses the <code>ThemeContext.Consumer</code> method:<br />

<div class="break-out">

 <pre><code class="language-javascript">import React, { Component } from "react";
import ThemeContext from "../Context/ThemeContext";
import AppTheme from "../Colors";

class Main extends Component {
    constructor() {
        super();
        this.state = {}
    }
    render() {
        return (
            &lt;ThemeContext.Consumer&gt;
                {
                    ([theme]) =&gt; {
                        const currentTheme = AppTheme[theme];
                        return(
                            &lt;main style = {{
                                padding: "1rem",
                                backgroundColor: `${currentTheme.backgroundColor}`,
                                color: `${currentTheme.textColor}`,
                            
                            }}&gt;
                                &lt;h1&gt;Heading 1&lt;/h1&gt;
                                &lt;p&gt;This is a paragraph&lt;/p&gt;
                                &lt;button&gt; This is a button&lt;/button&gt;
                            &lt;/main&gt;
                        )
                       
                    }
                }
            &lt;/ThemeContext.Consumer&gt;
        );
    }

}
export default Main;
</code></pre>
</div>
</li>
</ol>

### Editing Our `MainWithFunction` Component

The `MainWithFunction` Component should be edited as the following:

<pre><code class="language-javascript">import React, { useContext } from "react";
import ThemeContext from "../Context/ThemeContext";
import AppTheme from "../Colors";


const Main = () =&gt; {
    const theme = useContext(ThemeContext)[0];
    const currentTheme = AppTheme[theme];
    return(
        &lt;main style = {{
            padding: "1rem",
            backgroundColor: `${currentTheme.backgroundColor}`,
            color: `${currentTheme.textColor}`,        
        }}&gt;
            &lt;h1&gt;Heading 1&lt;/h1&gt;
            &lt;p&gt;This is a paragraph&lt;/p&gt;
            &lt;button&gt; This is a button&lt;/button&gt;
        &lt;/main&gt;
    );
}

export default Main;
</code></pre>

## Conclusion

That’s it! We have succeeded in implementing two theme modes for our React app using the Context API.

In the process, we have learned:

- What the Context API is and the problem it solves;
- When to use the Context API;
- Creating `Context` and consuming it in both functional and class-based components.

### <span class="rh">Further Reading</span> on SmashingMag:

<ul>
<li><a title="Read 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db3ed2a5-7a94-4bab-a9f5-275d1ca394f0/introduction-react-context-api.png'" href="https://www.smashingmagazine.com/2019/06/styling-modern-web-apps/" rel="bookmark">Styling In Modern Web Apps</a></li>
<li><a title="Read 'Building Mobile Apps With Ionic And React'" href="https://www.smashingmagazine.com/2019/08/building-mobile-apps-ionic-react/" rel="bookmark">Building Mobile Apps With Ionic And React</a></li>
<li><a title="Read 'Build A PWA With Webpack And Workbox'" href="https://www.smashingmagazine.com/2019/06/pwa-webpack-workbox/" rel="bookmark">Build A PWA With Webpack And Workbox</a></li>
<li><a title="Read 'Getting To Know The MutationObserver API'" href="https://www.smashingmagazine.com/2019/04/mutationobserver-api-guide/" rel="bookmark">Getting To Know The MutationObserver API</a></li>
</ul>

{{< signature "dm, il" >}}

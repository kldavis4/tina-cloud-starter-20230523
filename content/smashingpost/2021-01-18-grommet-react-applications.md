---
title: 'Using Grommet In React Applications'
slug: grommet-react-applications
author: fortune-ikechi
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d1826be-7095-4530-9f04-0bf140f3842f/grommet-react-applications.jpg
date: 2021-01-18T14:30:13.000Z
summary: >-
  In this tutorial, we’re going to learn how to use Grommet as a UI library for React applications. We’ll use Grommet as a UI library of choice to create a pricing component, this would help us have a better understanding of how to use Grommet.
description: >-
  In this tutorial, we’re going to learn how to use Grommet as a UI library for React applications. We’ll use Grommet as a UI library of choice to create a pricing component, this would help us have a better understanding of how to use Grommet.
categories:
  - React
  - UI
  - JavaScript
---

Over the years, the React ecosystem has grown with the invention of libraries that help the development of React applications. In this tutorial, we are going to learn to use [Grommet](https://v2.grommet.io/) for developing responsive, accessible, and mobile-first components for React applications. We’ll take a closer look at its core concepts, some of its use cases, and build a simple example. It’s important to note that Grommet is open-source with 6.9k stars on [GitHub](https://github.com/grommet/grommet).

This tutorial will be beneficial to readers who are interested in developing responsive components in their React application using Grommet. This article requires a basic understanding of React and Styled-components.

## What Is Grommet?

[Grommet](https://v2.grommet.io/) is a React component library that boasts of responsive and accessible mobile-first code components. It does this through its components &mdash; which are the building blocks for the library. They include Layouts, Types, Colors, Controls, Inputs, Visualizations Media and utilities. All grommet components are inbuilt with accessibility and responsiveness in mind. 

Grommet provides support for [W3C’s spec](https://www.w3.org/TR/WCAG21/) which makes it score a huge point in terms of accessibility. It also provides powerful themes and tools that allow you to customize your color, type, component elements and layout needs according to your project needs. 

Some popular alternatives to Grommet include [tailwindcss](https://tailwindcss.com/) and [styled components](https://styled-components.com/), although very popular among developers, each framework differ in approach in building applications. Grommet is mobile-first, accessible, responsive and themes out of the box and has support for W3C for easy creation of React applications while Tailwind CSS is a highly customizable and utility framework that allows developers to build applications without the restrictions of CSS such as its cascading rules. Styled-components aim to help developers write reusable React components by allowing us to write CSS code in our JavaScript using object literals and it also uses components as low-level styling construct. 

In our project, we will be using Grommet in our projects due to its customizable components, accessibility, and theme properties which we’d need as we go forward in this tutorial.

{{% feature-panel %}}

### Using Grommet Components

Grommet like so many other component libraries comes pre-built with some components for layouts and themes such as Box, Card and Header components. To use first you’d need to install the grommet package using NPM or yarn, like the code block below. 

<pre><code class="language-bash">npm i grommet styled-components</code></pre>

Or:

<pre><code class="language-bash">yarn add grommet styled-components</code></pre>

From the above, you can see that we also installed styled-components. This is because Grommet uses styled-components for customizing styles in components; it's advisable to install styled-components in your projects. 

To use a Grommet component in a React project, you need to import `grommet`. Let’s build a card component below to explain:

<pre><code class="language-javascript">import React from 'react';
import { Grommet, Card } from 'grommet';

export default function GrommetExample() {
  return (
     &lt;Card&gt;
        &lt;CardBody pad="medium"&gt;Body&lt;/CardBody&gt;
          &lt;Button
            icon={&lt;Icons.Favorite color="red" /&gt;}
              hoverIndicator
            /&gt;
        &lt;/Card&gt;
      );
    }</code></pre>

In the code block above, first imported `Grommet` and the `Card` component from `grommet` package into your file, next we wrapped our component using the `Card` component we’ve imported. Styles can be added to a Grommet component as objects like we did to the `Button` or they can be styled using styled-components. 

Let’s see more examples of Grommet components by looking at Form components.

## Why Grommet? 

Grommet's primary purpose is to improve the experience of developers and make for a faster way of building React applications with its mobile-first, accessible, and responsive components. Grommet seamlessly aligns a design and a developer workflow to create a seamless experience, making it very easy for anyone to get started with. 

Grommet also provides support for screen readers out of the box, theme variants such as dark-mode are gotten from grommet out of the box and they can be set up using the `themeMode` prop in a React application, like below.

<div class="break-out">

 <pre><code class="language-javascript">import React from "react";
import { Grommet, Box, Button, Heading, dark } from "grommet";
import { grommet } from "grommet";
const App = () =&gt; {
  const [darkMode, setDarkMode] = React.useState(false);
  return (
    &lt;Grommet full theme={grommet} themeMode={darkMode ? "dark" : "light"}&gt;
      &lt;Box pad="large"&gt;
        &lt;Heading level="1"&gt;Grommet Darkmode toggle&lt;/Heading&gt;
        &lt;Button
          label="Toggle Theme"
          primary
          alignSelf="center"
          margin="large"
          onClick={() =&gt; setDarkMode(!darkMode)}
        /&gt;
      &lt;/Box&gt;
    &lt;/Grommet&gt;
  );
};
export default App;</code></pre>
</div>

In the code block above, we are using the `themeMode` property to add a dark mode. Using a ternary operator, we check if the page is on dark mode, we can toggle it to light mode, next we added a button for toggling between the light and dark mode on our application, you can check here for a demo on [Codesandbox](https://codesandbox.io/s/gallant-wilson-o2s2b?file=/src/App.js).

Grommet can also exist with other frameworks and doesn’t add a global style that will affect existing components in your React application, functions and styles can be interpolated into an object literal for styles. Grommet also features Layout components, which features some CSS properties such as flexbox, it also takes in all flexbox properties as props. 

Grommet features a big library of SVG icons that are accessible using the `<Icon />` component, unlike many other frameworks. Grommet features components for data visualization such as bar charts, maps and even progress trackers. 

Several firms use Grommet today to create real-world applications, including Netflix, IBM, Sony, Samsung, Shopify, GitHub and Twilio.

{{% ad-panel-leaderboard %}}

## Building A Pricing Component With Grommet

Now we know the basics and core concepts of Grommet, we are going to create a pricing component using Grommet components, it should feature components such as Card, Box and Buttons from the Grommet library. 

Without further ado, let’s start!

## Setting Up Your Environment

First, let’s create a bare React application, write the code block below on your terminal.

<pre><code class="language-bash">create-react-app grommet-app</code></pre>

The above code will create a bare React application using the [create-react-app](https://github.com/facebook/create-react-app) package. Move into the project directory.

<pre><code class="language-bash">cd grommet-app</code></pre>

Next is to install the dependencies we’d need in our project.

<pre><code class="language-bash">yarn add grommet styled-components</code></pre>

If you’ve done this, then start the project server using the command below.

<pre><code class="language-bash">yarn start</code></pre>

For this project, we’d need a single component for our cards and style with styled-components.

Let’s create the first card below 

<pre><code class="language-javascript">import React from "react";
import styled from "styled-components";

export default function GrommetCard() {
  return (
    &lt;&gt;
       &lt;CardWrapper&gt;
        &lt;Card left&gt;
          &lt;Div&gt;
            &lt;Div&gt;
              &lt;CardContent&gt;
                &lt;small&gt;Basic&lt;/small&gt;
                &lt;h1&gt;$588&lt;/h1&gt;
              &lt;/CardContent&gt;
              &lt;CardContent&gt;
                &lt;p&gt;500 GB storage&lt;/p&gt;
              &lt;/CardContent&gt;
              &lt;CardContent&gt;
                &lt;p&gt;2 Users Allowed&lt;/p&gt;
              &lt;/CardContent&gt;
              &lt;CardContent&gt;
                &lt;p&gt;Send Up To 3 GB&lt;/p&gt;
              &lt;/CardContent&gt;
            &lt;/Div&gt;
            &lt;CardButton secondary&gt;LEARN MORE&lt;/CardButton&gt;
          &lt;/Div&gt;
        &lt;/Card&gt;
   &lt;/CardWrapper&gt;
    &lt;/&gt;
  );
}</code></pre>

In the code block above, we are using the component `CardWrapper` to wrap all of our `Card` components, next we added a new component, `CardContent` which is used to wrap all of our content in each card component. The `CardButton` component is a button component that is used on cards on Grommet. 

Next, let’s create styles for our application using styled-components. Write the file below:

<div class="break-out">

<pre><code class="language-javascript">const primaryGradient = "linear-gradient(hsl(236, 72%, 79%), hsl(237, 63%, 64%))";

const CardWrapper = styled.div&#96;
  display: flex;
  justify-content: center;
  align-items: center;
  height: max-content;
  margin: 20px;
  @media all and (max-width: 1240px) {
    flex-direction: column;
  }
&#96;;</code></pre>
</div>

In the above, we defined a style object for our `CardWrapper` in our application. Let’s add style objects for our Card component above.

<div class="break-out">

<pre><code class="language-javascript">const Card = styled.div`
  min-width: 380px;
  box-shadow: 3px -2px 19px 0px rgba(50, 50, 50, 0.51);
  border-radius: ${(props) =&gt; (props.left ? " 6px 0 0 6px" : props.right ? "0 6px 6px 0" : "6px")};
  background: ${(props) =&gt; (props.secondary === undefined ? "#fff" : primaryGradient)};
  padding: 25px 20px;
  height: ${(props) =&gt; (props.center ? "520px" : "480px")};
  display: flex;
  justify-content: center;
  align-items: center;
  @media all and (max-width: 1240px) {
    margin-bottom: 20px;
    border-radius: 6px;
    height: 480px;
  }
  @media all and (max-width: 420px) {
    min-width: 90%;
  }
`;</code></pre>
</div>

Let’s add more styles to our components.

<div class="break-out">

<pre><code class="language-javascript">const CardButton = styled.div`
  min-width: 100%;
  padding: 10px 15px;
  min-height: 50px;
  box-shadow: 1px 1px 0 rgba(0, 0, 0, 0.2), 0px 0px 2px rgba(0, 0, 0, 0.2);
  color: ${(props) =&gt; (props.secondary !== undefined ? "#fff" : "#7c7ee3")};
  background: ${(props) =&gt; (props.secondary === undefined ? "#fff" : primaryGradient)};
  text-align: center;
  margin-top: 25px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 600;
  font-size: 16px;
  border-radius: 6px;
`;
const CardContent = styled.div`
  width: 100%;
  color: ${(props) =&gt; (props.secondary !== undefined ? "#fff" : "#000")};
  padding-bottom: 10px;
  margin-bottom: 10px;
  border-bottom: 1.3px solid #eee;
  text-align: center;
`;
const Div = styled.div`
  min-width: 100%;
`;</code></pre>
</div>

Once we’ve done all this, our project should look similar to the image below.

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d260f2bd-6b7d-442b-8ad3-1f234e7bd432/4-grommet-react-applications.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d260f2bd-6b7d-442b-8ad3-1f234e7bd432/4-grommet-react-applications.png" sizes="100vw" caption="A Grommet card. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d260f2bd-6b7d-442b-8ad3-1f234e7bd432/4-grommet-react-applications.png'>Large preview</a>)" alt="A Grommet card" >}}

We need to add more cards to our component using the code block below.

<pre><code class="language-javascript"> &lt;Card center secondary&gt;
         &lt;Div&gt;
            &lt;Div&gt;
              &lt;CardContent secondary&gt;
                &lt;small&gt;Premium&lt;/small&gt;
                &lt;h1&gt;$788&lt;/h1&gt;
              &lt;/CardContent&gt;
              &lt;CardContent secondary&gt;
                &lt;p&gt;75 GB storage&lt;/p&gt;
              &lt;/CardContent&gt;
              &lt;CardContent secondary&gt;
                &lt;p&gt;4 Users Allowed&lt;/p&gt;
              &lt;/CardContent&gt;
              &lt;CardContent secondary&gt;
                &lt;p&gt;Send Up To 5 GB&lt;/p&gt;
              &lt;/CardContent&gt;
            &lt;/Div&gt;
            &lt;CardButton&gt;LEARN MORE&lt;/CardButton&gt;
          &lt;/Div&gt;
        &lt;/Card&gt;
        
       &lt;Card right&gt;
          &lt;Div&gt;
            &lt;Div&gt;
              &lt;CardContent&gt;
                &lt;small&gt;PRO&lt;/small&gt;
                &lt;h1&gt;$1000&lt;/h1&gt;
              &lt;/CardContent&gt;
              &lt;CardContent&gt;
                &lt;p&gt;1TB storage&lt;/p&gt;
              &lt;/CardContent&gt;
              &lt;CardContent&gt;
                &lt;p&gt;Unlimited Users Allowed&lt;/p&gt;
              &lt;/CardContent&gt;
              &lt;CardContent&gt;
                &lt;p&gt;Send Up To 10 GB&lt;/p&gt;
              &lt;/CardContent&gt;
            &lt;/Div&gt;
            &lt;CardButton secondary&gt;LEARN MORE&lt;/CardButton&gt;
          &lt;/Div&gt;
        &lt;/Card&gt;
      &lt;/CardWrapper&gt;
    &lt;/&gt;
  );
}
</code></pre>
    
Here, we created two more card components, adding our own custom components with styled-components and used the style objects we defined above to wrap our Grommet components and improve styling. 

Our final price card application should look like the image below.

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/568ff530-80c3-407f-94d3-20ecf068e67c/5-grommet-react-applications.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/568ff530-80c3-407f-94d3-20ecf068e67c/5-grommet-react-applications.png" sizes="100vw" caption="Grommet price card application. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/568ff530-80c3-407f-94d3-20ecf068e67c/5-grommet-react-applications.png'>Large preview</a>)" alt="Grommet price card application" >}}

{{% ad-panel-leaderboard %}}

## Using Grommet In Production (Building List App)

To see an example of what it’d look like using Grommet in another application, we are going to build a simple app that will allow a user to add, view and delete list items. We will be using in-built React Context API to manage the state of the application, Grommet for our UI components and styled-components for styling our application. 

Again, let’s initialize a react app using the command below.

<pre><code class="language-bash">create-react-app list-app</code></pre>

cd into the project directory

<pre><code class="language-bash">cd list-app</code></pre>

<pre><code class="language-bash">yarn add grommet grommet-controls grommet-icons styled-components</code></pre>

In the above code block, we installed:

<table class="tablesaw" data-tablesaw-mode="stack" data-tablesaw-minimap>
  <tbody>
    <tr>
      <td><code>grommet</code></td>
      <td>Our UI component library</td>
    </tr>
    <tr>
      <td><code>grommet-controls</code>, <code>grommet-icons</code></td>
      <td>Icons and controls packages we need to install to work with Grommet</td>
    </tr>
    <tr>
      <td><code>styled-components</code></td>
      <td>For utilizing tagged literals for styling react components and grommet</td>
    </tr>
  </tbody>
</table>

## Building The App Context

In the application we need to share the user’s data across multiple components, to achieve that we would make use of Context API. With this, we can create an App Context that would hold the lists and logic for our application. You can check out this [article](https://www.smashingmagazine.com/2020/01/introduction-react-context-api/) to learn more about Context API.

To create our app context, first create a folder called `context` in the `src` directory of our application, next create a file called `AppContext.js` this will be the file for all our app context, let’s do that in the code block below:

<pre><code class="language-javascript">import React, { createContext, useState } from 'react';
export const Context = createContext();
const AppContext = ({children}) =&gt; {
  const [lists, setLists] = useState([]);
  const removeList = item =&gt; {
    let newLists = [...lists];
    
    lists.map((list, id) =&gt; {
      return list === item && newLists.splice(id, 1);
    });
    setLists(newLists);
  }</code></pre>

In the code block above, we imported the context API hook `createContext` and the `useState` hook all from React, using the `useState` component, we created a central state for our application, this was done so that the component can act as a Context Provider for other components in our application. Next, we created a new variable named `removeList` that takes in an item as a parameter, using the spread operator we are spreading what’s in the state and splicing out the object that’s equal to the item we want to remove. 

Next, we will use the logic above to create methods for adding and deleting list items in our application, we do that in the code block below:

<pre><code class="language-javascript">return (
    &lt;Context.Provider value={{
      lists,
      addToLists: (newItem) =&gt; setLists([...lists, newItem]),
      deleteFromList: (item) =&gt; removeList(item)
    }}&gt;
      {children}
    &lt;/Context.Provider&gt;
  )
}
export default AppContext;</code></pre>

Here, we are returning the `Context.Provider` and accepting children props, we are doing this so that other component will be able to access the properties we pass in the value prop, we initialized the `lists` object to take in our lists, the `addToList` method takes in a `newItem` parameter to add new lists to our application state and the `deleteFromList` removes or deletes an item from the list store.

## Building The List Component 

In this section, we are going to build our List component using Grommet for our UI components and styled-components to style some parts of our UI. First, create a components folder inside our application `src` directory, then inside the components folder, create a new file `List.js` and inside it, write the code below.

<div class="break-out">

 <pre><code class="language-javascript">import React from "react";
import styled from "styled-components";
import { Card, CardBody, Box, Text, Button } from "grommet";
function List(props) {
  return (
    &lt;StyledDiv&gt;
      &lt;Card&gt;
        &lt;CardBody className="card_body"&gt;
          &lt;Box direction="row" className="item_box"&gt;
            &lt;Text className="text"&gt;{props.list}&lt;/Text&gt;
            &lt;Box className="button_box"&gt;
              &lt;Button
                onClick={props.deleteList.bind(this, props.list)}
                className="button"
              &gt;
                Delete
              &lt;/Button&gt;
            &lt;/Box&gt;
          &lt;/Box&gt;
        &lt;/CardBody&gt;
      &lt;/Card&gt;
    &lt;/StyledDiv&gt;
  );
}
export default List;</code></pre>
</div>

In the code above, we first imported components Card, CardBody, Box, Text and Button from grommet, next we created a List component to take in props, using Grommet components we created a card component with a delete button that will be automatically added to a list. Next is to style our component below: 

<pre><code class="language-css">const StyledDiv = styled.div`
  .button {
    background-color: #8b0000;
    color: white;
    padding: 10px;
    border-radius: 5px;
  }
  .card_body {
    padding: 20px;
    margin-top: 20px;
  }
  .item_box {
    justify-content: space-between;
  }
  .text {
    margin-top: auto;
    margin-bottom: auto;
  }
`;
</code></pre>

Once we do the above, our component should look like the image below.

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66a9062a-0330-4e4d-b0fe-a6f5652536b4/3-grommet-react-applications.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66a9062a-0330-4e4d-b0fe-a6f5652536b4/3-grommet-react-applications.png" sizes="100vw" caption="List component. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66a9062a-0330-4e4d-b0fe-a6f5652536b4/3-grommet-react-applications.png'>Large preview</a>)" alt="List component" >}}

## Building The List Display Component

This component displays all the lists we’ve added and also automatically generates a delete button as soon as a new list is added. 

<div class="break-out">

<pre><code class="language-javascript">import React from "react";
import List from "./List";
import { Context } from '../context/AppContext';
function ListDisplay() {
  return (
    &lt;Context.Consumer&gt;
      {(context) =&gt; (
        &lt;div className="container"&gt;
          {context.lists.length ? 
            context.lists.map((list, id) =&gt; (
              &lt;List key={id} list={list} deleteList={context.deleteFromList} /&gt;
            )) : null
          }
        &lt;/div&gt;
      )}
    &lt;/Context.Consumer&gt;
  );
}
export default ListDisplay;</code></pre>
</div>

In this component, we created a function `ListDisplay` and wrapped it using the `Context.Consumer` from our `appContext` component, next using a `div` for our container tag, we destructured the `list` and `deleteList` methods from the app context, by doing this we can be able to pass them as props. Next, we map through the `lists` to return a new list, which we can use in building a single list by passing the returned object as props to the `List` component. 

Our component should look like this with lists added:

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/368de418-1c3d-4eaa-8463-57ee6bb046ac/1-grommet-react-applications.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/368de418-1c3d-4eaa-8463-57ee6bb046ac/1-grommet-react-applications.png" sizes="100vw" caption="List display component. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/368de418-1c3d-4eaa-8463-57ee6bb046ac/1-grommet-react-applications.png'>Large preview</a>)" alt="list display component" >}}

## NavBar Component

This component will be the bulk of our application, here we will wrao our component using the `Context.Consumer` and similar to our other components, we will be styling with styled components for styling. Let’s build this component below.

<div class="break-out">

 <pre><code class="language-javascript">import React, { useState } from "react";
import { Heading, Form, TextInput, Button } from "grommet";
import styled from "styled-components";
import { Context } from '../context/AppContext';
function Navbar() {
  const [value, setValue] = useState("");
  return (
    &lt;Context.Consumer&gt;
      {store =&gt; (
        &lt;StyledDiv className="container"&gt;
          &lt;Heading className="title"&gt;Grommet List App&lt;/Heading&gt;
          &lt;Form onSubmit={() =&gt; store.addToLists(value)} className="form-group"&gt;
            &lt;TextInput
              className="form"
              value={value}
              type="text"
              onChange={(e) =&gt; setValue(e.target.value)}
              placeholder="Enter item"
            /&gt;
            &lt;Button type='submit' className="button">Add to List&lt;/Button&gt;
          &lt;/Form&gt;
        &lt;/StyledDiv&gt;
      )}
    &lt;/Context.Consumer&gt;
  );
}
const StyledDiv = styled.div`
  .button {
    margin-top: 10px;
    background-color: purple;
    color: white;
    padding: 10px;
    border-radius: 5px;
  }
`;
export default Navbar;
</code></pre>
</div>

First, in order to access the properties in the application context provider, we wrapped our component in a `Context.Consumer` component. Next, we added a `Heading` tag from Grommet, and then we created an input form for adding our lists by using the method `addToList` which takes in a value parameter (in our case the value is the user’s input). Last but not least, we added a Submit button to handle the form submit. 

Once done correctly, our app should look like this:

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87ca0ae8-4f01-4792-a735-cef9a9e4d883/2-grommet-react-applications.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87ca0ae8-4f01-4792-a735-cef9a9e4d883/2-grommet-react-applications.png" sizes="100vw" caption="Grommet list app. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87ca0ae8-4f01-4792-a735-cef9a9e4d883/2-grommet-react-applications.png'>Large preview</a>)" alt="grommet list app" >}}

## Conclusion

In this article, we learned about Grommet, a component library with responsiveness and accessibility in mind. We also went through the process of creating a pricing component application using Grommet and a list application. Have fun using Grommet for your component and UI needs for your next React application. The code for the Grommet list application can be found on [Codesandbox](https://codesandbox.io/s/affectionate-shape-scpeq?file=/src/components/navbar.js) and the pricing component can be found [here](https://codesandbox.io/s/zen-thompson-8r5xc?file=/src/App.js).

### Resources

- [Grommet docs](https://v2.grommet.io/)
- [An introduction to Grommet](https://medium.com/@ddarrowphl/grommet-5a6c5accd45e)
- [Introduction to React’s Context API](https://www.smashingmagazine.com/2020/01/introduction-react-context-api/)

{{< signature "ks, vf, yk, il" >}}

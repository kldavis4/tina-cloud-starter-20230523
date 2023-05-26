---
title: 'Compound Components In React'
slug: compound-components-react
author: ichoku-chinonso
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9df8cb4-b274-407a-97a8-f06488571802/compound-components-react.jpg
date: 2021-08-27T13:00:00.000Z
summary: >-
  A compound component is one of the advanced patterns of React which makes use of an interesting way to communicate the relationship between UI components and share implicit state by leveraging an explicit parent-child relationship.
description: >-
  Compound components help developers build more expressive and flexible APIs to share state and logic within components. This tutorial explains how this can be achieved with the help of using the Context API and React to build components by using this advanced pattern.
categories:
  - API
  - React
  - Tools
  - Techniques
---

Compound components help developers build more expressive and flexible APIs to share state and logic within components. This tutorial explains how this can be achieved with the help of using the Context API and React to build components by using this advanced pattern. 

**Note**: *In order to be able to follow along, you’ll need a basic understanding of React and how the Context API works.*

## What Is A Compound Component?

Compound components can be said to be a pattern that encloses the state and the behavior of a group of components but still gives the rendering control of its variable parts back to the external user.

From the definition above, taking note of the keywords: **state** and **behavior**. This helps us understand that compound component deal with state (i.e. how state behaves across a component which is enclosed by an external user being the parent of the component).

The objective of compound components is to provide a more expressive and flexible API for communication between the parent and the child components.

Think of it like the `<select>` and `<option>` tags in HTML:

<pre><code class="language-html">&lt;select&gt;
  &lt;option value="volvo"&gt;Volvo&lt;/option&gt;
  &lt;option value="mercedes"&gt;Mercedes&lt;/option&gt;
  &lt;option value="audi"&gt;Audi&lt;/option&gt;
&lt;/select&gt;</code></pre>
  
The `select` tag works together with the `option` tag which is used for a drop-down menu to select items in HTML. Here the `<select>` manages the state of the UI, then the `<option>` elements are configured on how the `<select>` should work. Compound components in React are used to build a declarative UI component which helps to avoid prop drilling.

Prop drilling is passing props down multiple child components. This is also what they call a “code smell”. The worst part of prop drilling being that when the parent component re-renders, the child components will also re-render and cause a domino effect on the component. A good solution would be to use the React Context API which we will also look into later.

{{% feature-panel %}}

## Applying Compound Components In React

This section explains the packages we can make use of in our application which adopt the compound component pattern of building components in React. This example is a [`Menu`](https://reach.tech/menu-button) component from the `@reach` UI package.

<pre><code class="language-javascript">import {
  Menu,
  MenuList,
  MenuButton,
  MenuItem,
  MenuItems,
  MenuPopover,
  MenuLink,
} from "@reach/menu-button";
import "@reach/menu-button/styles.css";</code></pre>

Here’s a way you can use the `Menu` component:

<pre><code class="language-javascript">function Example() {
  return (
    &lt;Menu&gt;
      &lt;MenuButton&gt;Actions&lt;/MenuButton&gt;
      &lt;MenuList&gt;
        &lt;MenuItem&gt;Download&lt;/MenuItem&gt;
        &lt;MenuLink to="view"&gt;View&lt;/MenuLink&gt;
      &lt;/MenuList&gt;
    &lt;/Menu&gt;
  );
}</code></pre>

The example code above is one of the implementations of compound components in which you get to see that the `Menu`, `MenuButton`,`MenuList`, `MenuItem` and `MenuLink` were all imported from `@reach/menu-button`. As opposed to exporting a single component, ReachUI exports a parent component which is `Menu` accompanying its children components which are the `MenuButton`, `MenuList`, `MenuItem` and the `MenuLink`.

## When Should You Make Use Of Compound Components?

As a React developer, you should make use of compound components when you want to:

- Solve issues related to building reusable components;
- Development of highly cohesive components with minimal coupling;
- Better ways to share logic between components.

## Pros And Cons Of Compound Components

A compound component is an awesome React pattern to add to your React developer toolkit. In this section, I’ll state the pros and cons of using compound components and what I have learned from building components using this pattern of development.

### Pros 

- **Separation Of Concern**  
Having all the UI state logic in the parent component and communicating that internally to all the child components makes for a clear division of responsibility.

- **Reduced Complexity**  
As opposed to prop drilling to pass down properties to their specific components, child props go to their respective child components using the compound component pattern.

### Cons

One of the major cons of building components in React with the compound component pattern is that only `direct children` of the parent component will have access to the props, meaning we can’t wrap any of these components in another component.

<pre><code class="language-javascript">export default function FlyoutMenu() {
  return (
    &lt;FlyOut&gt;
      {/* This breaks */}
      &lt;div&gt;
        &lt;FlyOut.Toggle /&gt;
        &lt;FlyOut.List&gt;
          &lt;FlyOut.Item&gt;Edit&lt;/FlyOut.Item&gt;
          &lt;FlyOut.Item&gt;Delete&lt;/FlyOut.Item&gt;
        &lt;/FlyOut.List&gt;
      &lt;/div&gt;
    &lt;/FlyOut&gt;
  );
}</code></pre>

A solution to this issue would be to use the flexible compound component pattern to implicitly share state using the `React.createContext` API.

Context API makes it possible to pass React state through nested components when building using the compound component pattern of building components in React. This is possible because `context` provides a way to pass data down the component tree without having to pass props down manually at every level.  Making use of Context API provides loads of flexibility to the end-user.

### Maintaining Compound Components In React

Compound components provide a more flexible way to share state within React applications, so making use of compound components in your React applications makes it easier to maintain and actually debug your apps.

{{% ad-panel-leaderboard %}}

## Building A Demo

In this article, we are going to build an accordion component in React using the compound components pattern. The component we are going to be building in this tutorial would be a **custom-made accordion component** that is flexible and shares state within the component by using the Context API.

Let’s go!

First of all, let’s create a React app by using the following:

<pre><code class="language-bash">npx create-react-app accordionComponent
cd accordionComponent
npm start</code></pre>

or

<pre><code class="language-bash">yarn create react-app accordionComponent
cd accordionComponent
yarn start</code></pre>

The commands above create a React app, change the directory to the React project, and start up the development server.

**Note**: *In this tutorial, we will be making use of `styled-components` to help style our components.*

Use the command below to install `styled-components`:

<pre><code class="language-bash">yarn add styled-components</code></pre>

or

<pre><code class="language-bash">npm install --save styled-components</code></pre>

In the **src** folder, create a new folder called  **components**. This is where all our components would live. Within the **components** folder, create two new files: `accordion.js` and `accordion.styles.js`.

The `accordion.styles.js` file contains our styling for the `Accordion` component (our styling was done using `styled-components`).

<pre><code class="language-javascript">import styled from "styled-components";

export const Container = styled.div`
  display: flex;
  border-bottom: 8px solid #222;
`;</code></pre>

Above is an example of styling components using the `css-in-js` library called `styled-components`.

Within the `accordion.styles.js` file, add the remaining styles:

<pre><code class="language-javascript">export const Frame = styled.div`
  margin-bottom: 40px;
`;
export const Inner = styled.div`
  display: flex;
  padding: 70px 45px;
  flex-direction: column;
  max-width: 815px;
  margin: auto;
`;
export const Title = styled.h1`
  font-size: 40px;
  line-height: 1.1;
  margin-top: 0;
  margin-bottom: 8px;
  color: black;
  text-align: center;
`;
export const Item = styled.div`
  color: white;
  margin: auto;
  margin-bottom: 10px;
  max-width: 728px;
  width: 100%;
  &:first-of-type {
    margin-top: 3em;
  }
  &:last-of-type {
    margin-bottom: 0;
  }
`;
export const Header = styled.div`
  display: flex;
  flex-direction: space-between;
  cursor: pointer;
  margin-bottom: 1px;
  font-size: 26px;
  font-weight: normal;
  background: #303030;
  padding: 0.8em 1.2em 0.8em 1.2em;
  user-select: none;
  align-items: center;
  img {
    filter: brightness(0) invert(1);
    width: 24px;
    user-select: none;
    @media (max-width: 600px) {
      width: 16px;
    }
  }
`;
export const Body = styled.div`
  font-size: 26px;
  font-weight: normal;
  line-height: normal;
  background: #303030;
  white-space: pre-wrap;
  user-select: none;
  overflow: hidden;
  &.closed {
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.25ms cubic-bezier(0.5, 0, 0.1, 1);
  }
  &.open {
    max-height: 0px;
    transition: max-height 0.25ms cubic-bezier(0.5, 0, 0.1, 1);
  }
  span {
    display: block;
    padding: 0.8em 2.2em 0.8em 1.2em;
  }
`;</code></pre>

Let’s start building our accordion component. In the `accordion.js` file, let’s add the following code:

<pre><code class="language-javascript">import React, { useState, useContext, createContext } from "react";
import {
  Container,
  Inner,
  Item,
  Body,
  Frame,
  Title,
  Header
} from "./accordion.styles";</code></pre>

Above, we are importing the `useState`, `useContext` and the `createContext` hooks which will help us to build our accordion component using compound components. 

The [React documentation](https://reactjs.org/docs/context.html) explains that `context` helps provide a way to pass data through the component tree without having to pass props down manually at every level.

Looking at what we have imported earlier in our `accordion.js` file, you will notice that we also imported our styles as components which will help us build our components faster.

We will go ahead and create our context for the component which will share data with the components that need them:

<pre><code class="language-javascript">const ToggleContext = createContext();
export default function Accordion({ children, ...restProps }) {
  return (
    &lt;Container {...restProps}&gt;
      &lt;Inner&gt;{children}&lt;/Inner&gt;
    &lt;/Container&gt;
  );
}</code></pre>

The `Container` and the `Inner` components from the above code snippet are from our `./accordion.styles.js` file in which we created styles for our components using the `styled-components` (from the `css-in-js` library). The `Container` component houses the whole `Accordion` we are building by using compound components.

Here we are creating a context object using the `createContext()` method, so when React renders a component that subscribes to this Context object, it will read the current context value from the closest matching Provider above it in the tree.

Then we are also creating our base component which is the Accordion; it takes the `children` and any `restProps`. This is our parent component which houses the children components of the Accordion.

Let’s create other children components within the `accordion.js` file:

<pre><code class="language-javascript">Accordion.Title = function AccordionTitle({ children, ...restProps }) {
  return &lt;Title {...restProps}&gt;{children}&lt;/Title&gt;;
};
Accordion.Frame = function AccordionFrame({ children, ...restProps }) {
  return &lt;Frame {...restProps}&gt;{children}&lt;/Frame&gt;;
};</code></pre>

Notice the `.` after the parent Accordion component; this is used to connect the child component to its parent component.

Let’s continue. Now add the following to the `accordion.js` file:

<pre><code class="language-javascript">Accordion.Item = function AccordionItem({ children, ...restProps }) {
  const [toggleShow, setToggleShow] = useState(true);
  return (
    &lt;ToggleContext.Provider value={{ toggleShow, setToggleShow }}&gt;
      &lt;Item {...restProps}&gt;{children}&lt;/Item&gt;
    &lt;/ToggleContext.Provider&gt;
  );
};
Accordion.ItemHeader = function AccordionHeader({ children, ...restProps }) {
  const { isShown, toggleIsShown } = useContext(ToggleContext);
  return (
    &lt;Header onClick={() =&gt; toggleIsShown(!isShown)} {...restProps}&gt;
      {children}
    &lt;/Header&gt;
  );
};
Accordion.Body = function AccordionHeader({ children, ...restProps }) {
  const { isShown } = useContext(ToggleContext);
  return (
    &lt;Body className={isShown ? "open" : "close"}&gt;
      &lt;span&gt;{children}&lt;/span&gt;
    &lt;/Body&gt;
  );
};</code></pre>

So here we are creating a `Body`, `Header` and `Item` component which are all children of the parent component `Accordion`. This is where it might start to get tricky. Also, notice that each child component created here also receives a `children` prop and `restprops`.

From the `Item` child component, we initialized our state using the `useState` hook and set it true. Then also remember that we created a `ToggleContext` at the top level of `accordion.js` file which is a `Context Object`, and when React renders a component that subscribes to this Context object, it will read the current context value from the closest matching Provider above it in the tree.

Every Context object comes with a `Provider` React component that allows consuming components to subscribe to context changes.

The `provider` component accepts a `value` prop to be passed to consuming components that are descendants of this provider, and here we are passing the current state value which is the `toggleShow` and method to set the value of the current state `setToggleShow`. They are the value that determines how our context object will share state around our component without prop drilling.

Then in our `header` child component of the `Accordion`, we are destructing the values of the context object, then changing the current state of the `toggleShow` on click. So what we are trying to do is to hide or show our accordion when the Header is clicked on.

In our `Accordion.Body` component, we are also destructing the `toggleShow` which is the current state of the component, then depending on the value of `toggleShow`, we can either hide the body or show the contents of the `Accordion.Body` component.

So that’s all for our `accordion.js` file.

Now this is where we get to see how everything we have learned about `Context` and `Compound components` come together. But before that, let’s create a new file called `data.json` and paste the content below into it:

<pre><code class="language-javascript">[
  {
    "id": 1,
    "header": "What is Netflix?",
    "body": "Netflix is a streaming service that offers a wide variety of award-winning TV programs, films, anime, documentaries and more – on thousands of internet-connected devices.\n\nYou can watch as much as you want, whenever you want, without a single advert – all for one low monthly price. There’s always something new to discover, and new TV programs and films are added every week!"
  },
  {
    "id": 2,
    "header": "How much does Netflix cost?",
    "body": "Watch Netflix on your smartphone, tablet, smart TV, laptop or streaming device, all for one low fixed monthly fee. Plans start from £5.99 a month. No extra costs or contracts."
  },
  {
    "id": 3,
    "header": "Where can I watch?",
    "body": "Watch anywhere, anytime, on an unlimited number of devices. Sign in with your Netflix account to watch instantly on the web at netflix.com from your personal computer or on any internet-connected device that offers the Netflix app, including smart TVs, smartphones, tablets, streaming media players and game consoles.\n\nYou can also download your favorite programs with the iOS, Android, or Windows 10 app. Use downloads to watch while you’re on the go and without an internet connection. Take Netflix with you anywhere."
  },
  {
    "id": 4,
    "header": "How do I cancel?",
    "body": "Netflix is flexible. There are no annoying contracts and no commitments. You can easily cancel your account online with two clicks. There are no cancellation fees – start or stop your account at any time."
  },
  {
    "id": 5,
    "header": "What can I watch on Netflix?",
    "body": "Netflix has an extensive library of feature films, documentaries, TV programs, anime, award-winning Netflix originals, and more. Watch as much as you want, any time you want."
  }
]</code></pre>

This is the data we will be working with in order to test our accordion component.

So let’s keep going. We are almost through and I believe you have learned a lot from following this article.

In this section, we are going to bring together everything we have been working on and learning about compound components to be able to use it in our `App.js` file to use the `Array.map` function to display the data we already have on the web page. Also notice that there was no use of state within the `App.js`; all we did was pass down data to the specific components and Context API took care of every other thing.

Now on to the final part. In your `App.js`, do the following:

<pre><code class="language-javascript">import React from "react";
import Accordion from "./components/Accordion";
import faqData from "./data";
export default function App() {
  return (
    &lt;Accordion&gt;
      &lt;Accordion.Title&gt;Frequently Asked Questions&lt;/Accordion.Title&gt;
      &lt;Accordion.Frame&gt;
        {faqData.map((item) =&gt; (
          &lt;Accordion.Item key={item.id}&gt;
            &lt;Accordion.Header&gt;{item.header}&lt;/Accordion.Header&gt;
            &lt;Accordion.Body&gt;{item.body}&lt;/Accordion.Body&gt;
          &lt;/Accordion.Item&gt;
        ))}
      &lt;/Accordion.Frame&gt;
    &lt;/Accordion&gt;
  );
}</code></pre>

In your **App.js** file, we imported our Compound Component Accordion from the file path, then also imported our dummy data, mapped through the dummy data in order to get the individual items in our data file, then displayed them in accordance with the respective component, also you would notice that all we had to do was to pass the children to the respective component, the Context API takes care of ensuring that it reaches the right component and there was no prop drilling.

This is what our final product should look like:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be245a08-912e-4671-bc03-b848761398aa/accordion-component.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be245a08-912e-4671-bc03-b848761398aa/accordion-component.png" width="800" height="477" sizes="100vw" caption="Final Look of our Accordion Component. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be245a08-912e-4671-bc03-b848761398aa/accordion-component.png'>Large preview</a>)" alt="Final Look of our Accordion Component" >}}

{{% ad-panel-leaderboard %}}

## Alternative To Compound Components

An alternative to using compound components would be to make use of the Render Props API. The term [Render Prop](https://reactjs.org/docs/render-props.html) in React refers to a technique for sharing code between React components using a prop whose value is a function. A component with a render prop takes a function that returns a React element and calls it instead of implementing its own render logic.

To pass data from a component down to a child component that needs the data may result to prop drilling when you have components nested within each other. This is the advantage of using Context to share data between components over using the render prop method.

## Conclusion

In this article, we learned about one of the advanced patterns of React which is the compound component pattern. It’s an awesome method to build reusable components in React by using the compound component pattern to build your component offers you a lot of flexibility in your component. You can still opt to make use of [Render Prop](https://reactjs.org/docs/render-props.html) if flexibility is not what your component requires at the moment. 

Compound components are most helpful in building [design systems](https://github.com/jbranchaud/awesome-react-design-systems). We also went through the process of sharing the state within the components using the Context API.

- The code for this tutorial can be found on [Codesandbox](https://codesandbox.io/s/trusting-wind-8ixc9?file=/src/components/Accordion.js).

{{< signature "ks, vf, yk, il" >}}

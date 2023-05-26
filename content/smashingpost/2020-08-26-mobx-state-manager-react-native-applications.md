---
title: 'Using Mobx As A State Manager In React Native Applications'
slug: mobx-state-manager-react-native-applications
author: fortune-ikechi
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aee2bf87-676a-4b01-98a0-17dbc997f1e8/mobx-state-manager-react-native-applications.png
date: 2020-08-26T11:00:00.000Z
summary: >-
  MobX is one of the many state management tools available to React developers. In this tutorial, Fortune Kay explains what MobX is and how you can use it in your React applications by building one from scratch.
description: >-
  MobX is one of the many state management tools available to React developers. In this tutorial, we’re going to learn how to use MobX to manage state in React Native applications by building a React Native application to see how this is done.
categories:
  - Apps
  - Native
  - React
  - MobX
---

State management is an integral part of developing JavaScript applications especially React and React Native applications. In this tutorial, we are going to learn how to use the MobX library for state management; understand the core concepts, some use cases and build a simple example. 

**Note:** *Basic knowledge of Javascript and React Native will be of great benefit as you work through this tutorial.*

## Using MobX In React Applications 

State is the data that your component(s) is working with &mdash; it holds the data that a component requires and it dictates what a component renders. State management is the process of managing how the state gets updated and passed from one component to another. Monitoring and working with data in an application can be difficult and that’s the need for state management libraries. Handling all the data for your application can be a little daunting especially when your application grows in size and complexity, building your own state management tool is not just time-consuming but difficult, This is why you might want to use a state management library.

However, it is important to know that state isn’t the only data that a component renders, components can also render props passed down to it. 
 
## Options For State Management

State management libraries for React Native applications include; [React Context API](https://www.smashingmagazine.com/2020/01/introduction-react-context-api/), [Redux](https://www.smashingmagazine.com/2018/07/redux-designers-guide/), MobX and [Unstated Next](https://blog.logrocket.com/state-management-with-unstated-next/).  

Although these state managers each have their advantages and disadvantages, I personally recommend MobX because of its simplicity, minimal boilerplate code &mdash; it doesn’t require you change your code, this is because in its core, MobX is and looks like JavaScript; you don’t need a change of architecture to support it (unlike Redux and to a lesser extent Context).

In fact it’s such an invisible abstraction that in many cases if you take out all of the MobX code &mdash; the *@observable*, *@computed*, *@action* and *observer* decorators, your code will work exactly the same (though it’ll have some performance issues) and it’s not limited to a global state. These are some reasons to go forward with MobX as a state manager of choice for your React Native applications.

Although it’s also important to note some issues with using MobX as a state manager, some of which include its avoidance of rules on how to implement it and MobX can be difficult to debug especially when you change state directly in a component without using the `@actions` parameter.

## What Is MobX?

According to the [official documentation](https://mobx.js.org/README.html), MobX is a battle-tested library that makes state management simple and scalable by transparently applying functional reactive programming. MobX treats your application like a spreadsheet. The logic is that *Anything that can be derived from the application state, should be done automatically*. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef57e66c-2fd4-4a3e-beee-c270dc05040b/5-using-mobx-state-manager-react-native-applications.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef57e66c-2fd4-4a3e-beee-c270dc05040b/5-using-mobx-state-manager-react-native-applications.png" sizes="100vw" caption="MobX state architecture. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef57e66c-2fd4-4a3e-beee-c270dc05040b/5-using-mobx-state-manager-react-native-applications.png'>Large preview</a>)" alt="MobX state architecture" >}}

{{% feature-panel %}}

## Core Principles And Concept Of MobX

MobX differentiates itself from other state managers with the following concepts.

### 1. State

State is the data your application holds &mdash; it’s roughly the entire contents of its memory. This also applies to your components.

### 2. Derivations

In MobX, anything that can be derived from the state without interactions is a derivation. Examples of derivations include:

- User interface,
- Backend add-ons such as changes to a server.

MobX has two mains types of derivations:

- **Computed values**  
Computed values are mostly values that can be derived from a current state using pure functions.
- **Reactions**  
Reactions in derivations are side effects that happen as a results of changes in your application state. They are similar to a computed value, but instead of producing a new value, a reaction produces a side effect for things like printing to the console, making network requests, incrementally updating the React component tree to patch the DOM, and so on.

A golden rule when using MobX is that when creating a value based on the current state, use a computed value. 

### 3. Actions

Unlike derivations, actions are code that cause changes to an application state &mdash; code that changes the state. They are anything that modifies the state. With MobX you can make it explicit in your code, Actions are mostly user events such as inputs, backend data pushes or even scheduled events. 

To better understand Actions, let’s look at an example from the [MobX documentation](https://mobx.js.org/refguide/action.html).

<pre><code class="language-javascript">class Ticker {
    @observable tick = 0

    @action
    increment() {
        this.tick++ // 'this' will always be correct
    }
}

const ticker = new Ticker()
setInterval(ticker.increment, 1000)</code></pre>   
   
Here, we set an `@observable` tick with an initial value of 0. Next, we created a function increment that is also an action that updates the initial value once a tick is made every second. 

## Observables In MobX

Observables or observable values in MobX are mostly JavaScript primitives, plain objects, classes, arrays and maps. They’re mostly used by first declaring an observable and adding a value to it and then calling it by adding an @observable as shown below:

<pre><code class="language-javascript">  observable(value)
 @observable classProperty = value</code></pre>

## Store Architecture Approach In MobX 

MobX principal architecture includes parts and ideas such as services, store, view models and containers &mdash; some of which are explained below. 

- **Service**  
This is usually a function called from a container; they can be used to get data from APIs and be added to the store. 
- **Store**  
As the name implies, this is the central place of the state used by an application. Usually in MobX, these include the observables, variables, actions and computed properties. 
- **Container**  
This calls `service` and puts data from View Model to View Component as React **props** (should be marked with `@observer` decorator).

{{% ad-panel-leaderboard %}}

## MobX In React And Native Applications

For learning purposes, in this tutorial, we are going to build a simple list app that will allow a user to add, view, and delete list items. We will be using MobX as a state manager in this application to add lists, update and delete them from the app state. However, it’s important to note that you already understand the basic concepts of JavaScript and React. 

Without further ado, let’s start! 

## Setting Up Your Environment

Now that we know how what MobX is and how it works, let me walk you through setting up your project. 

First, let’s create a project with the following, write the following code on your terminal to initialise a project:

<pre><code class="language-bash">npx create-react-app listapp</code></pre>

The above code will create a bare React application using the [create-react-app](https://github.com/facebook/create-react-app) package. Move into the project directory:

<pre><code class="language-bash">cd listapp</code></pre>

For this app, we will need three components: 

- `TitleInput`  
This will contain the title for our project and an input form for adding lists. 
- `List`  
This will be an input form that would allow a user to add a list. It will have an add button to add our list items. 
- `ListsDisplay`  
This component will display all of the user list items and also a delete button that’s automatically generated when a user adds a list item. 

We will use a Store.js to contain the app state and methods to modify it similar to Redux. Let’s outline what they will be used for. 

- `mobx`  
This is the state manager we will be using for this project.
- `mobx-react`  
This is the official React bindings for MobX.
- `bootstrap`  
We will be using bootstrap version 4.5 to style our project.
- `uuid`  
This is used to automatically create keys for deleting lists.

Having done that, let’s go ahead and install these packages. I will be installing them with an npm alternative done in yarn:

<pre><code class="language-bash">yarn add mobx mobx-react bootstrap@4.5.0 uuid</code></pre>

Once the packages are installed, we will start our app in development mode by running the code below in our terminal:

<pre><code class="language-bash">yarn start</code></pre>

## Setting Up Our App Store 

Let’s create a store for our project. First, create a file in the root directory of our project called **ListStore**, this will be the central location of our app state. 

For this app, we will need to create a **ListStore** in order not to repeat ourselves when we use it in other app components.

<div class="break-out">

<pre><code class="language-javascript">/*** src/Store.js ***/

import { observable, action, computed } from "mobx";
import { v4 } from "uuid";

export class List {
  @observable value
  @observable done

  constructor (value) {
    this.id = v4()
    this.value = value
  }
}

export class ListStore {
  @observable lists = []
  @observable filter = ""
  @action addList = (value) =&gt; {
    this.lists.push(new List(value))
  }
 
  @action deleteList = (list) =&gt; {
    this.lists = this.lists.filter(t =&gt; t !== list)
  }
  @computed get filteredLists () {
    const matchCase = new RegExp(this.filter, "i")
    return this.lists.filter(list=&gt; !this.filter || matchCase.test(list.value))
  }
}</code></pre>   
</div>

In the code above, we imported three functions from `mobx`.

- `observable`  
This holds a variable which can be updated in the event of a change in state.
- `action`  
Used to modify the application state.
- `computed`  
Values that can be derived from the existing state or other computed values, it changes after a state gets modified. 

The class `List` has two object values which are `done` and `value` which will hold the initial state of the app and the modification in the case of changes. 

We want our new list to automatically create a key so that we can automatically get a delete button once a list is created, Here uuid is used to automatically create keys in our application.

Next, we added an `addList` function that will add lists when clicked by using the `.push()` method to *push* the list in the array we already created in the `@observable lists` array.

The `deleteList` function accepts `List` as a property which is supposed to be the item the user wants to remove. Then we set the value of `this.Lists` to a new array after we have removed the selected item.

Both `addLists` and `deleteList` are actions because they modify the state of our app when changes are made. 

{{% ad-panel-leaderboard %}}

## Initializing The MobX Store

Next on our list is to import our store in our **App.js** and use it in our project. 

<pre><code class="language-javascript">import React from 'react';
import Navbar from "./components/navbar";
import ListDisplay from "./components/ListDisplay";
import {ListStore} from './ListStore';
function App() {
  const store = new ListStore()
  return (
    &lt;div&gt;
      &lt;Navbar store={store}/&gt;
      &lt;ListDisplay store={store}/&gt;
    &lt;/div&gt;
  );
}
export default App;</code></pre>
    

Here we imported the **TitleInput** and **ListDisplay** components. Then we initialized the store in our `App.js` in order to be able to pass it as props to the **TitleInput** and **ListDisplay** components. 

Normally this will throw an error because we’ve not worked on the other components, so let’s do that. Let’s build out the `ListDisplay` component. 

## `ListDisplay`

This component displays all of our added lists and also automatically generates a delete button once a new list is added. 

<pre><code class="language-javascript">import React from 'react'

import List from "./List";
import { observer } from 'mobx-react';

function ListDisplay(props) {
  const { deleteList, filteredLists } = props.store

  return (
    &lt;div>
        &lt;div className="container"&gt;
          {filteredLists.map(list =&gt; (
            &lt;List key={list.id} 
              list={list}  
                deleteList={deleteList} 
            /&gt;
          ))}
        &lt;/div&gt;
    &lt;/div&gt;
  )
}
export default observer(ListDisplay)</code></pre>
    
For this component, we created a function `ListDisplay` and made it an observer, we also destructure the `list` and `deletelist` functions from the store, by doing this, we made it easier to pass then as object props.

Next, we map through `filteredLists` to return the lists, which we then use in building the individual list by passing the returned item as props to the **List** component.

Once done, our component should look like this with lists added:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30f7a23d-885d-4475-b2f3-5a27791b41ec/1-using-mobx-state-manager-react-native-applications.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30f7a23d-885d-4475-b2f3-5a27791b41ec/1-using-mobx-state-manager-react-native-applications.png" sizes="100vw" caption="Lists displayed by `ListDisplay` component. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30f7a23d-885d-4475-b2f3-5a27791b41ec/1-using-mobx-state-manager-react-native-applications.png'>Large preview</a>)" alt="The list display component" >}}

Next is to add a **List** and **TitleInput** components.

## List Component

Just like our other components, our `List` component will export the list as an observer in order to help the store watch it for changes. 

<pre><code class="language-javascript">import React from 'react'
import { observer } from 'mobx-react'
function List(props) {
  return (
    &lt;div className="card"&gt;
      &lt;div className="card-body"&gt;
          &lt;div className="d-flex justify-content-between 
          align-items-center"&gt;
            &lt;p className={`title ${props.list.done 
              ? "text-secondary" : ""}`}&gt;
              {props.list.value}
              &lt;/p&gt;
            &lt;div&gt;
            &lt;button 
              onClick={props.deleteList.bind(this, props.list)} 
                className="btn btn-danger 
                  font-weight-bold py-2 px-5 ml-2"&gt;
                Delete
              &lt;/button&gt;
            &lt;/div&gt;
          &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  )
}
export default observer(List)</code></pre>

I used the bootstrap to create cards in the first set of `divs` and also align the delete icon to move towards the right-hand side of the app. First, we created a card component to handle our `list` and then we created a button tag for the delete `button` that will accept two objects of this and pass a prop to the list, this will on click, will remove the selected list item from the lists in the page. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb4c5a62-77cf-4322-9255-f259bd1bbe7a/2-using-mobx-state-manager-react-native-applications.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb4c5a62-77cf-4322-9255-f259bd1bbe7a/2-using-mobx-state-manager-react-native-applications.png" sizes="100vw" caption="A single list component with the delete button. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb4c5a62-77cf-4322-9255-f259bd1bbe7a/2-using-mobx-state-manager-react-native-applications.png'>Large preview</a>)" alt="The list component" >}}

Next is to our **TitleInput** which will contain our input form for adding lists and the title for the project. 

## `TitleInput`

Similar to our other projects, we will be adding an `@observer` function so that the component will be able to accept props from the app Store. 

<div class="break-out">

 <pre><code class="language-javascript">
import React, { useState } from 'react'
import { observer } from 'mobx-react'
function Navbar(props) {
  const [value, setValue] = useState("")
  
  const {addList} = props.store
  const prepareAddList = (e) =&gt; {
    e.preventDefault()
    addList(value)
    setValue("")
  }
  return (
    &lt;div className="container mt-3"&gt;
      &lt;h1 className="title"&gt;List App&lt;/h1&gt;
      &lt;form onSubmit={prepareAddList} className="form-group"&gt;
          &lt;div className="row ml-lg-2"&gt;
            &lt;input className="form-control-lg col-12 col-lg-9 
              col-sm-12 mr-3 border border-secondary" 
                value={value} type="text" onChange={(e) =&gt; 
                  setValue(e.target.value)} placeholder="Enter list"
                  /&gt;
                   &lt;button className="col-lg-2 col-5 col-sm-5 mt-2 
                  mt-lg-0 mt-sm-2 btn btn-lg btn-success 
                font-weight-bold"&gt;
              Add to List
            &lt;/button&gt;
          &lt;/div&gt;
      &lt;/form&gt;
     &lt;/div&gt;
  )
}
export default observer(Navbar)</code></pre>
</div>

First, we initialized an initial state. Using React Hooks, we added an initial state called `values` which we set to an empty string. We use this to hold the value of what is entered in the input field. To know more about React Hooks, you can check out [this article](https://www.smashingmagazine.com/2020/04/react-hooks-best-practices/) by David Abiodun.

Then we called an object for adding lists to the store `addList` and passed it as props from the app store.

Next we created a function `preparedAddList` to accept an event object for the input forms, we also added a button for adding the lists manually on click. 

Almost done, we need to restart our project server by running:

<pre><code class="language-bash">yarn start</code></pre>

And our `TitleInput` should look like this:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7e6d224-98a2-4b96-9f67-8b33a38cf79c/4-using-mobx-state-manager-react-native-applications.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7e6d224-98a2-4b96-9f67-8b33a38cf79c/4-using-mobx-state-manager-react-native-applications.png" sizes="100vw" caption="Title and input component. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7e6d224-98a2-4b96-9f67-8b33a38cf79c/4-using-mobx-state-manager-react-native-applications.png'>Large preview</a>)" alt="A title input" >}}

We are now done with all of our app components, so let’s assemble it in our `App.js`. To do that, we need to import our components `titleInput` and `ListDisplay`. We also need to import our store from the Store component.

In order for MobX to work in our App, we need to pass the MobX store as props in our App and individual components so that they get the properties and functions in the store. 

<pre><code class="language-javascript">import React from 'react';
import Navbar from "./components/navbar";
import ListDisplay from "./components/ListDisplay";
import {ListStore} from './ListStore';
function App() {
  const store = new ListStore()
  return (
    &lt;div&gt;
      &lt;Navbar store={store}/&gt;
      &lt;ListDisplay store={store}/&gt;
    &lt;/div&gt;
  );
}
export default App;</code></pre>

Our app should look like this when completed:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6078e2a-0591-402c-9a5d-bd9445451038/3-using-mobx-state-manager-react-native-applications.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6078e2a-0591-402c-9a5d-bd9445451038/3-using-mobx-state-manager-react-native-applications.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6078e2a-0591-402c-9a5d-bd9445451038/3-using-mobx-state-manager-react-native-applications.png'>Large preview</a>)" alt="Completed list app" >}}

## Conclusion

MobX is a great state manager especially for React-based applications, building our list app, we’ve learned the basic concepts of MobX, state, derivations, and actions. A working version of this app can be found [here](https://codesandbox.io/s/iamfortunelistapp-tc1pn):

<iframe loading="lazy" src="https://codesandbox.io/embed/github/iamfortune/listapp/tree/master/?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="iamfortune/listapp"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

You can take this further by using MobX in the next application you build that involves the management of state. I’d love to see what new things you come up with. You can read more on MobX and state management applications in the references below. 

### Resources And References

- “[React Native with MobX — Getting Started](https://medium.com/react-native-training/react-native-with-mobx-getting-started-ba7e18d8ff44),” Nader Dabit, Medium
- “[Concepts & Principles](https://mobx.js.org/intro/concepts.html)” MobX (official documentation)
- “[Best Practices With React Hooks](https://www.smashingmagazine.com/2020/04/react-hooks-best-practices/),” Adeneye David Abiodun, Smashing Magazine

{{< signature "ks, ra, yk, il" >}}
